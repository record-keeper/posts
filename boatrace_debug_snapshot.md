# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-09T13:50:02.172024+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×45  [2026-10-09T13:04:54]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×11  [2026-10-09T12:31:20]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×6  [2026-10-09T11:07:01]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-10-09T10:00:16]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-09T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-09T06:00:24]
- key: `ORPHAN_SCAN|166 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-09T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-09T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S00: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-10-09T06:00:24]
- key: `ROI_STAT|S00: n=166 hit%=25.9% hit_CI[Bonf]=[17.4,36.7]% ROI=0.67 ROI_boot95=[0.47,0.89]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-09T06:00:24]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=31.9% hit_CI[Bonf]=[22.5,43.1]% ROI=1.00 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-09T06:00:24]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=46.3% hit_CI[Bonf]=[31.5,61.8]% ROI=0.80 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-09T06:00:24]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=41.4% ROI=1.10 (コスト 8,300/回収 9,150)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-09T06:00:24]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=26.0% ROI=0.66 (コスト 11,800/回収 7,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-09T06:00:24]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=90 hit%=32.2% ROI=0.86 (コスト 20,400/回収 17,610)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-09T06:00:24]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=47 hit%=38.3% ROI=0.85 (コスト 11,000/回収 9,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-09T06:00:24]
- key: `DRIFT_BUCKET|drift ≥+30%: n=44 hit%=22.7% ROI=0.69 (コスト 11,500/回収 7,920)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-09T06:00:24]
- key: `CALIBRATION_LIVE|bt=win: n=411 pred=0.4819 actual=0.3236 error=+0.1583 (+33%) brier=0.2511 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-09T06:00:24]
- key: `CALIBRATION_LIVE|S00(win): n=166 pred=0.4534 hit=0.2590 cal_err=+0.1944 brier=0.2514 BSS=-0.31 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-09T06:00:24]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=163 pred=0.4909 hit=0.3190 cal_err=+0.1718 brier=0.2465 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-09T06:00:24]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=82 pred=0.5219 hit=0.4634 cal_err=+0.0584 brier=0.2598 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.28MB / last modified 2026-10-09T13:49:52.441032+09:00

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
S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-09 13:49:03,973 [INFO] predictor: Models loaded OK
2026-10-09 13:49:15,018 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=08&hd=20261009: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-09 13:49:26,054 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=08&hd=20261009: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-09 13:49:38,471 [WARNING] scraper: beforeinfo parse failed: jcd=08 rno=8
2026-10-09 13:49:38,471 [WARNING] run_cycle: fetch None: 08/8
2026-10-09 13:49:41,917 [INFO] scraper: odds3t: 120/120 parsed
2026-10-09 13:49:43,056 [INFO] scraper: odds3f: 20/20 parsed
2026-10-09 13:49:44,145 [INFO] scraper: odds2t: 30/30 parsed
2026-10-09 13:49:44,147 [INFO] scraper: odds2f: 15/15 parsed
2026-10-09 13:49:45,224 [INFO] scraper: odds_win: 6/6 parsed
2026-10-09 13:49:45,224 [INFO] scraper: fetch_race 03/7: boats=6 odds=191/191
2026-10-09 13:49:45,228 [INFO] predictor: CALIBRATION_MODE=on
2026-10-09 13:49:45,228 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-09 13:49:45,232 [INFO] run_cycle: fetched 03/7 [scan]: 156 combos
2026-10-09 13:49:48,709 [INFO] scraper: odds3t: 120/120 parsed
2026-10-09 13:49:49,798 [INFO] scraper: odds3f: 20/20 parsed
2026-10-09 13:49:50,932 [INFO] scraper: odds2t: 30/30 parsed
2026-10-09 13:49:50,933 [INFO] scraper: odds2f: 15/15 parsed
2026-10-09 13:49:52,032 [INFO] scraper: odds_win: 5/6 parsed
2026-10-09 13:49:52,032 [INFO] scraper: fetch_race 10/8: boats=6 odds=190/191
2026-10-09 13:49:52,034 [INFO] predictor: CALIBRATION_MODE=on
2026-10-09 13:49:52,034 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-09 13:49:52,038 [INFO] run_cycle: fetched 10/8 [scan]: 155 combos
2026-10-09 13:49:52,173 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 58
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 58
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 12, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 89
  FINAL_MISSING: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 38 | 18 | 11,400 | 13,830 | +2,430 | 1.213 |
| S01_NAKAANA1 | 39 | 19 | 7,800 | 12,520 | +4,720 | 1.605 |
| S02_TETSUBAN | 18 | 6 | 3,600 | 2,080 | -1,520 | 0.578 |

## 直近アラート (24h・新しい順)
```
[13:47:32] FINAL_MISSING: {"deadline": "2026-10-09T13:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100923101317", "sid": "S00"}
[13:40:39] FINAL_MISSING: {"deadline": "2026-10-09T13:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100905061310", "sid": "S00"}
[13:04:53] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:03:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1016}
[13:02:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1038}
[13:01:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1033}
[13:00:47] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1034}
[12:59:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1005}
[12:36:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1065}
[12:35:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1072}
```

## 本日残レース: 82件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 62件 締切済
- 通知発射: scan=9 nid / final=10 nid / result=5 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 165R | win | 1 | 0.3177 | 4.9 | 1.56 | 300 | scan=- drift=- | 12:53:19 |
| S00 | 163R | win | 1 | 0.5891 | 4.1 | 2.42 | 300 | scan=- drift=- | 11:54:29 |
| S00 | 032R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=7.7 drift=-48.1% | 11:38:51 |
| S00 | 162R | win | 1 | 0.5174 | 9.0 | 4.66 | 300 | scan=7.5 drift=+20.0% | 11:26:19 |
| S01_NAKAANA1 | 022R | win | 1 | 0.5719 | 3.2 | 1.83 | 200 | scan=3.6 drift=-11.1% | 11:13:20 |
| S01_NAKAANA1 | 1611R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=3.2 drift=-6.2% | 16:12:42 |
| S02_TETSUBAN | 1610R | win | 1 | 0.5891 | 2.8 | 1.65 | 200 | scan=- drift=- | 15:37:19 |
| S00 | 1610R | win | 1 | 0.5891 | 5.6 | 3.30 | 300 | scan=5.8 drift=-3.4% | 15:36:29 |
| S01_NAKAANA1 | 168R | win | 1 | 0.5123 | 4.2 | 2.15 | 200 | scan=3.7 drift=+13.5% | 14:19:19 |
| S00 | 088R | win | 1 | 0.5719 | 11.5 | 6.58 | 300 | scan=9.9 drift=+16.2% | 13:38:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +4.9% | -68.9% | +169.2% | 22 | 7 | 46 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 525.3s |
| **Latency** (scan→final max) | 646.6s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 409 | 0.4821 | 0.3276 | +0.1545 | 🟡+32% | 0.2515 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4544 | 0.2651 | 0.2529 | 🔴-0.30 | 0.689 |
| S01_NAKAANA1 | win | 162 | 0.4905 | 0.3210 | 0.2459 | 🔴-0.13 | 1.015 |
| S02_TETSUBAN | win | 81 | 0.5221 | 0.4691 | 0.2599 | 🔴-0.04 | 0.812 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 157 | 0.4226 | 0.2930 | 🔴+0.1296 |
| 0.50+ | 237 | 0.5432 | 0.3502 | 🔴+0.1930 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 171 | 0.77 |
| win | <5.0 | ✅learned | 310 | 0.764 |
| win | <10.0 | ✅learned | 137 | 0.455 |
| win | <20.0 | ✅learned | 39 | 0.243 |
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
_auto-generated by claude_snapshot.py at 2026-10-09T13:50:02.172024+09:00_