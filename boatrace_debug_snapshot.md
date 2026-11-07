# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-07T13:20:01.321533+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×31 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×47 (24h)
- 🔴 PSI_DRIFT_DETECTED×31 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×3  [2026-11-07T13:08:42]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×3  [2026-11-07T13:08:42]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-07T13:00:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-11-07T12:51:55]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×10  [2026-11-07T12:37:27]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-07T12:30:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-07T11:30:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×12  [2026-11-07T10:01:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-07T09:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-07T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=58<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-07T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=152<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-07T06:00:12]
- key: `ORPHAN_SCAN|180 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-07T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=159<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-07T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2290 actual=0.1111 gap=+0.1179`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-07T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1878 actual=0.0000 gap=+0.1878`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-07T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=37.1% ROI=0.99 (コスト 7,900/回収 7,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-07T06:00:12]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=16.7% ROI=0.50 (コスト 9,600/回収 4,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-11-07T06:00:12]
- key: `ROI_STAT|S00: n=152 hit%=27.6% hit_CI[Bonf]=[18.5,39.1]% ROI=0.77 ROI_boot95=[0.54,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-07T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=159 hit%=33.3% hit_CI[Bonf]=[23.6,44.7]% ROI=0.82 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-07T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=58 hit%=46.6% hit_CI[Bonf]=[29.3,64.7]% ROI=1.07 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.62MB / last modified 2026-11-07T13:16:53.645755+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
696 [INFO] scraper: odds3f: 20/20 parsed
2026-11-07 13:18:29,708 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=7&jcd=05&hd=20261107: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-07 13:18:39,812 [INFO] scraper: odds2t: 30/30 parsed
2026-11-07 13:18:39,813 [INFO] scraper: odds2f: 15/15 parsed
2026-11-07 13:18:50,825 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=7&jcd=05&hd=20261107: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-07 13:19:01,859 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=7&jcd=05&hd=20261107: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-07 13:19:14,881 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=7&jcd=05&hd=20261107: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-07 13:19:14,881 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/oddstf?rno=7&jcd=05&hd=20261107
2026-11-07 13:19:14,881 [INFO] scraper: fetch_race 05/7: boats=6 odds=185/191
2026-11-07 13:19:14,885 [INFO] predictor: CALIBRATION_MODE=on
2026-11-07 13:19:14,885 [INFO] predictor: combos: {'2t': 30, '3t': 120}
2026-11-07 13:19:14,889 [INFO] run_cycle: fetched 05/7 [scan]: 150 combos
2026-11-07 13:19:26,300 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=02&hd=20261107: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-07 13:19:47,661 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=7&jcd=02&hd=20261107: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 22
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 22
  }
]
```

## Phase別通知記録 (24h)
{'final': 7, 'result': 5, 'scan': 10}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 256
  FINAL_MISSING: 47
  PSI_DRIFT_DETECTED: 31
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  LARGE_ODDS_DRIFT: 3
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 9 | 1 | 2,700 | 1,230 | -1,470 | 0.456 |
| S01_NAKAANA1 | 17 | 9 | 3,400 | 5,320 | +1,920 | 1.565 |
| S02_TETSUBAN | 9 | 1 | 1,800 | 220 | -1,580 | 0.122 |

## 直近アラート (24h・新しい順)
```
[13:16:52] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 330, "n_recent": 35, "psi": 0.906}
[13:16:52] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 12, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 477}
[13:12:23] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 332, "n_recent": 35, "psi": 0.906}
[13:12:23] FINAL_MISSING: {"deadline": "2026-11-07T11:39:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110702031139", "sid": "S00"}
[13:12:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 12, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 474}
[13:08:41] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:08:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 12, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 476}
[13:02:10] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 11, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 477}
[12:54:59] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 483}
[12:51:51] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 479}
```

## 本日残レース: 75件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 57件 締切済
- 通知発射: scan=6 nid / final=4 nid / result=2 nid
- predictions: 2 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 113R | win | 1 | 0.5174 | 7.6 | 3.93 | 300 | scan=6.8 drift=+11.8% | 11:22:13 |
| S02_TETSUBAN | 111R | win | 1 | 0.5719 | 2.6 | 1.49 | 200 | scan=2.3 drift=+13.0% | 10:26:11 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5735 | 3.8 | 2.18 | 200 | scan=3.4 drift=+11.8% | 16:33:25 |
| S01_NAKAANA1 | 153R | win | 1 | 0.5174 | 4.5 | 2.33 | 200 | scan=- drift=- | 16:11:12 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 12:59:37 |
| S01_NAKAANA1 | 109R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 12:35:37 |
| S02_TETSUBAN | 039R | win | 1 | 0.5998 | 2.1 | 1.26 | 200 | scan=2.8 drift=-25.0% | 14:29:45 |
| S02_TETSUBAN | 214R | win | 1 | 0.5476 | 2.3 | 1.26 | 200 | scan=- drift=- | 09:52:27 |
| S01_NAKAANA1 | 197R | win | 1 | 0.4994 | 3.4 | 1.70 | 200 | scan=3.5 drift=-2.9% | 20:23:15 |
| S01_NAKAANA1 | 194R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=4.6 drift=-17.4% | 19:01:10 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 16 | -4.1% | -51.3% | +25.0% | 5 | 1 | 10 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 414.1s |
| **Latency** (scan→final max) | 662.9s |
| **Traffic** (notifications 24h) | 22 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 365 | 0.4772 | 0.3233 | +0.1539 | 🟡+32% | 0.2330 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 150 | 0.4363 | 0.2600 | 0.2175 | 🔴-0.13 | 0.748 |
| S01_NAKAANA1 | win | 156 | 0.4873 | 0.3333 | 0.2373 | 🔴-0.07 | 0.821 |
| S02_TETSUBAN | win | 59 | 0.5544 | 0.4576 | 0.2610 | 🔴-0.05 | 1.056 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 9 | 0.2290 | 0.1111 | 🔴+0.1179 |
| 0.30-0.50 | 133 | 0.4141 | 0.3008 | 🔴+0.1133 |
| 0.50+ | 211 | 0.5457 | 0.3649 | 🔴+0.1807 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 198 | 0.809 |
| win | <5.0 | ✅learned | 367 | 0.744 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 47 | 0.249 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-11-07T13:20:01.321533+09:00_