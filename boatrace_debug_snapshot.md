# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-29T12:40:01.785960+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×43 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×43 (24h)
- 🟡 FINAL_MISSING×40 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×2  [2026-06-29T12:17:38]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 KS_ODDS_DRIFT  ×14  [2026-06-29T12:05:42]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CIRCUIT_BREAKER_TRIP  ×37  [2026-06-29T12:01:38]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×37  [2026-06-29T12:01:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×37  [2026-06-29T12:01:38]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-06-29T12:01:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-29T11:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-06-29T10:34:31]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ORPHAN_SCAN  ×1  [2026-06-29T06:00:13]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-29T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=139<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-29T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3217 actual=0.2381 gap=+0.0837`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-29T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1819 actual=0.3333 gap=-0.1514`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-29T06:00:13]
- key: `ROI_STAT|S00: n=163 hit%=27.6% hit_CI[Bonf]=[18.8,38.6]% ROI=0.72 ROI_boot95=[0.52,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-29T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-29T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=139 hit%=30.2% hit_CI[Bonf]=[20.4,42.3]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-29T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=75 hit%=30.7% hit_CI[Bonf]=[17.9,47.3]% ROI=0.48 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-29T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=75<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-29T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=25.7% ROI=0.83 (コスト 10,100/回収 8,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-29T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=22.9% ROI=0.49 (コスト 8,300/回収 4,030)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-29T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=83 hit%=30.1% ROI=0.71 (コスト 19,600/回収 13,950)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.39MB / last modified 2026-06-29T12:39:41.377528+09:00

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
-06-29 12:38:43,618 [INFO] run_cycle: SCAN S01_NAKAANA1 戸田5R A
2026-06-29 12:38:43,855 [INFO] run_cycle: run_cycle done: 2 notifications
2026-06-29 12:39:07,248 [INFO] run_cycle: === run_cycle 12:39:07 ===
2026-06-29 12:39:07,249 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-29 12:39:07,249 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-29 12:39:07,303 [INFO] predictor: Models loaded OK
2026-06-29 12:39:18,388 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=11&hd=20260629: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-29 12:39:30,078 [INFO] scraper: odds3t: 120/120 parsed
2026-06-29 12:39:31,275 [INFO] scraper: odds3f: 20/20 parsed
2026-06-29 12:39:32,377 [INFO] scraper: odds2t: 30/30 parsed
2026-06-29 12:39:32,378 [INFO] scraper: odds2f: 15/15 parsed
2026-06-29 12:39:33,460 [INFO] scraper: odds_win: 5/6 parsed
2026-06-29 12:39:33,460 [INFO] scraper: fetch_race 11/5: boats=6 odds=190/191
2026-06-29 12:39:33,472 [INFO] predictor: CALIBRATION_MODE=on
2026-06-29 12:39:33,472 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-29 12:39:33,480 [INFO] run_cycle: fetched 11/5 [final]: 155 combos
2026-06-29 12:39:37,265 [INFO] scraper: odds3t: 120/120 parsed
2026-06-29 12:39:38,396 [INFO] scraper: odds3f: 20/20 parsed
2026-06-29 12:39:39,612 [INFO] scraper: odds2t: 30/30 parsed
2026-06-29 12:39:39,613 [INFO] scraper: odds2f: 13/15 parsed
2026-06-29 12:39:40,843 [INFO] scraper: odds_win: 4/6 parsed
2026-06-29 12:39:40,843 [INFO] scraper: fetch_race 21/10: boats=6 odds=187/191
2026-06-29 12:39:40,853 [INFO] predictor: CALIBRATION_MODE=on
2026-06-29 12:39:40,853 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-29 12:39:40,861 [INFO] run_cycle: fetched 21/10 [scan]: 154 combos
2026-06-29 12:39:40,988 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 80
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 80
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 16, 'scan': 35}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 208
  PSI_DRIFT_DETECTED: 43
  FINAL_MISSING: 40
  CIRCUIT_BREAKER_TRIP: 26
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  KS_ODDS_DRIFT: 6
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 11 | 14,100 | 8,070 | -6,030 | 0.572 |
| S01_NAKAANA1 | 35 | 14 | 7,000 | 7,340 | +340 | 1.049 |
| S02_TETSUBAN | 7 | 2 | 1,400 | 600 | -800 | 0.429 |

## 直近アラート (24h・新しい順)
```
[12:38:43] FINAL_MISSING: {"deadline": "2026-06-29T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062903031208", "sid": "S00"}
[12:35:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1327}
[12:22:32] CIRCUIT_BREAKER_TRIP: {"cost": 14100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 47, "payout": 8070, "roi_7d": 0.572, "sid": "S00"}
[12:22:32] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 285, "n_recent": 89, "psi": 0.256}
[12:19:26] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 285, "n_recent": 88, "psi": 0.254}
[12:17:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1322}
[12:09:25] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.008521, "ks_stat": 0.199}
[12:09:25] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 285, "n_recent": 87, "psi": 0.26}
[12:05:41] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.009389, "ks_stat": 0.197}
[12:05:41] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 286, "n_recent": 87, "psi": 0.255}
```

## 本日残レース: 119件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 61件 締切済
- 通知発射: scan=14 nid / final=13 nid / result=5 nid
- predictions: 8 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 109R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=5.4 drift=-24.1% | 12:22:21 |
| S01_NAKAANA1 | 174R | win | 1 | 0.5990 | 3.5 | 2.10 | 200 | scan=- drift=- | 12:19:22 |
| S01_NAKAANA1 | 033R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=4.5 drift=+2.2% | 12:05:36 |
| S00 | 108R | win | 1 | 0.5123 | 4.8 | 2.46 | 300 | scan=- drift=- | 11:48:22 |
| S01_NAKAANA1 | 032R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=4.5 drift=-22.2% | 11:38:34 |
| S01_NAKAANA1 | 021R | win | 1 | 0.4989 | 4.5 | 2.25 | 200 | scan=3.7 drift=+21.6% | 10:44:46 |
| S00 | 021R | win | 1 | 0.4989 | 4.5 | 2.25 | 300 | scan=5.2 drift=-13.5% | 10:44:45 |
| S02_TETSUBAN | 216R | win | 1 | 0.5719 | 2.2 | 1.26 | 200 | scan=2.6 drift=-15.4% | 10:41:33 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5123 | 3.6 | 1.84 | 200 | scan=3.3 drift=+9.1% | 17:10:35 |
| S00 | 012R | win | 1 | 0.2290 | 8.6 | 1.97 | 300 | scan=18.3 drift=-53.0% | 15:59:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | +22.1% | -67.9% | +482.2% | 20 | 9 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 463.7s |
| **Latency** (scan→final max) | 624.8s |
| **Traffic** (notifications 24h) | 80 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 372 | 0.4800 | 0.2984 | +0.1816 | 🟡+38% | 0.2433 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 157 | 0.4402 | 0.2866 | 0.2303 | 🔴-0.13 | 0.756 |
| S01_NAKAANA1 | win | 139 | 0.4897 | 0.3094 | 0.2435 | 🔴-0.14 | 0.827 |
| S02_TETSUBAN | win | 76 | 0.5444 | 0.3026 | 0.2699 | 🔴-0.28 | 0.474 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 11 | 0.2269 | 0.0909 | 🔴+0.1360 |
| 0.30-0.50 | 127 | 0.4265 | 0.2598 | 🔴+0.1667 |
| 0.50+ | 220 | 0.5442 | 0.3318 | 🔴+0.2124 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 48 | 0.732 |
| win | <5.0 | ✅learned | 105 | 0.725 |
| win | <10.0 | ✅learned | 60 | 0.489 |
| win | <20.0 | ✅learned | 18 | 0.212 |
| win | <50.0 | ⚠️fallback | 2 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-29T12:40:01.785960+09:00_